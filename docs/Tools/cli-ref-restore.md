---
title: Polecenie restore NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia restore nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dd0a74c9ed9b879643ed24cbddacff87310dfd6b
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="restore-command-nuget-cli"></a>polecenie Restore (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 2.7 +

Pobiera i instaluje wszystkie pakiety brakuje `packages` folderu. W przypadku użycia z NuGet 4.0 + i PackageReference format, generuje `<project>.nuget.props` pliku, w razie potrzeby w `obj` folderu. (Plik można pominąć z kontroli źródła).

Mac OS x i Linux z poziomu interfejsu wiersza polecenia na Mono Przywracanie pakietów nie jest obsługiwany z PackageReference.

## <a name="usage"></a>Użycie

```cli
nuget restore <projectPath> [options]
```

gdzie `<projectPath>` Określa lokalizację rozwiązania lub `packages.config` pliku. Zobacz [uwagi](#remarks) poniżej behawioralnej szczegółowe informacje.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| DirectDownload | *(4.0 +)*  Pobiera pakiety bezpośrednio, bez wypełnianie pamięci podręczne z plików binarnych lub metadanych. |
| DisableParallelProcessing | Wyłącza Przywracanie wielu pakietów równolegle. |
| FallbackSource | *(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| MSBuildPath | *(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia. Obsługiwane wartości to 4, 12, 14, 15. Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild. |
| NoCache | Zapobiega przy użyciu pamięci podręcznej pakietów NuGet. Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie jest określony, używany jest bieżący folder. Wymagana, gdy przywrócenie za pomocą `packages.config` pliku, chyba że `PackagesDirectory` lub `SolutionDirectory` jest używany.|
| PackageSaveMode | Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`. |
| PackagesDirectory | Taki sam jak `OutputDirectory`. Wymagana, gdy przywrócenie za pomocą `packages.config` pliku, chyba że `OutputDirectory` lub `SolutionDirectory` jest używany. |
| Project2ProjectTimeOut | Limit czasu w sekundach dla rozpoznawania odwołań projektu do projektu. |
| Cykliczne | *(4.0 +)*  Przywraca wszystkie projekty odwołań dla projektów uniwersalnych systemu Windows i .NET Core. Nie ma zastosowania do projektów przy użyciu `packages.config`. |
| RequireConsent | Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów. Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder rozwiązania. Nieprawidłowy gdy trwa przywracanie pakietów dla rozwiązania. Wymagana, gdy przywrócenie za pomocą `packages.config` pliku, chyba że `PackagesDirectory` lub `OutputDirectory` jest używany. |
| Źródło | Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby przywracania. W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md). |
| Szczegółowość |> określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="remarks"></a>Uwagi

Polecenie restore wykonuje następujące czynności:

1. Określ tryb działania polecenia restore.

   | Typ pliku projectPath | Zachowanie |
   | --- | --- |
   | Rozwiązania (folder) | Wyszukuje NuGet `.sln` pliku i korzysta z jeśli je znaleziono; w przeciwnym razie zwraca błąd. `(SolutionDir)\.nuget` jest używana jako folder początkowy. |
   | `.sln` Plik | Przywracanie pakietów zidentyfikowane przez rozwiązanie; Zwraca błąd, jeśli `-SolutionDirectory` jest używany. `$(SolutionDir)\.nuget` jest używana jako folder początkowy. |
   | `packages.config` lub pliku projektu | Przywróć pakiety wymienione w pliku rozwiązania i instalowanie zależności. |
   | Innego typu pliku | Plik zakłada się, że `.sln` plik jako powyżej; Jeśli nie jest to rozwiązanie zapewnia NuGet błąd. |
   | (nie określono projectPath) | <ul><li>NuGet wyszukuje pliki rozwiązania w bieżącym folderze. Jeśli zostanie znaleziony jeden plik, że jeden służy do przywracania pakietów; w przypadku znalezienia wielu rozwiązań NuGet zawiera błąd.</li><li>Jeśli nie ma żadnych plików rozwiązania, NuGet szuka `packages.config` i użyty pod kątem przywracania pakietów.</li><li>Jeśli żadne rozwiązanie lub `packages.config` plik zostanie znaleziony, NuGet zawiera błąd.</ul> |

2. Określ folder pakietów przy użyciu następującej kolejności priorytet (NuGet zwraca błąd, jeśli żadnego z tych folderów nie są znaleziono):

    - Folder określony za pomocą `-PackagesDirectory`.
    - `repositoryPath` Vale w `Nuget.Config`
    - Folder określony za pomocą `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Trwa przywracanie pakietów dla rozwiązania, NuGet wykonuje następujące czynności:
    - Ładuje plik rozwiązania.
    - Przywraca poziomu pakietów rozwiązania na liście `$(SolutionDir)\.nuget\packages.config` do `packages` folderu.
    - Przywracanie pakietów na liście `$(ProjectDir)\packages.config` do `packages` folderu. Dla każdego pakietu określony Przywracanie pakietu równolegle, chyba że `-DisableParallelProcessing` jest określona.

## <a name="examples"></a>Przykłady

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
