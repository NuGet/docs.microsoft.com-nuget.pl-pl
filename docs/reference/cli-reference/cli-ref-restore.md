---
title: Polecenie przywracania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia przywracania NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328295"
---
# <a name="restore-command-nuget-cli"></a>Restore — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : 2.7+

Pobiera i instaluje wszystkie brakujące pakiety w `packages` folderze. W przypadku użycia z pakietem NuGet 4.0 + i formatem PackageReference program `<project>.nuget.props` generuje plik, w razie konieczności, w folderze.`obj` (Plik można pominąć z kontroli źródła).

W systemach Mac OSX i Linux przy użyciu interfejsu wiersza polecenia w systemie mono przywracanie pakietów nie jest obsługiwane z PackageReference.

## <a name="usage"></a>Użycie

```cli
nuget restore <projectPath> [options]
```

gdzie `<projectPath>` określa lokalizację rozwiązania `packages.config` lub pliku. Aby uzyskać szczegółowe informacje o zachowaniu, zobacz [uwagi](#remarks) poniżej.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| DirectDownload | *(4.0 +)* Pobiera pakiety bezpośrednio bez wypełniania pamięci podręcznych za pomocą jakichkolwiek plików binarnych lub metadanych. |
| DisableParallelProcessing | Wyłącza przywracanie równolegle wielu pakietów. |
| FallbackSource | *(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| MSBuildPath | *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo `-MSBuildVersion`przed. |
| MSBuildVersion | *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild. |
| NoCache | Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie zostanie określony, używany jest bieżący folder. Wymagane w przypadku przywracania z `packages.config` plikiem, `PackagesDirectory` chyba `SolutionDirectory` że lub jest używany.|
| PackageSaveMode | Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`lub `nuspec;nupkg`. |
| PackagesDirectory | Analogicznie `OutputDirectory`jak. Wymagane w przypadku przywracania z `packages.config` plikiem, `OutputDirectory` chyba `SolutionDirectory` że lub jest używany. |
| Project2ProjectTimeOut | Limit czasu w sekundach dla rozpoznawania odwołań między projektami. |
| cykliczne | *(4.0 +)* Przywraca wszystkie projekty odwołań dla projektów platformy UWP i .NET Core. Nie dotyczy projektów korzystających z `packages.config`programu. |
| RequireConsent | Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów. Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder rozwiązania. Nieprawidłowy podczas przywracania pakietów dla rozwiązania. Wymagane w przypadku przywracania z `packages.config` plikiem, `PackagesDirectory` chyba `OutputDirectory` że lub jest używany. |
| Source | Określa listę źródeł pakietów (jako adresy URL) do użycia podczas przywracania. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="remarks"></a>Uwagi

Polecenie Restore wykonuje następujące czynności:

1. Określ tryb operacji przywracania.

   | Typ pliku projectPath | Zachowanie |
   | --- | --- |
   | Rozwiązanie (folder) | Pakiet NuGet szuka `.sln` pliku i używa go, jeśli został znaleziony; w przeciwnym razie wystąpi błąd. `(SolutionDir)\.nuget`jest używany jako folder początkowy. |
   | `.sln`rozszerzeniem | Przywróć pakiety zidentyfikowane przez rozwiązanie; występuje błąd, jeśli `-SolutionDirectory` jest używany. `$(SolutionDir)\.nuget`jest używany jako folder początkowy. |
   | `packages.config`lub plik projektu | Przywróć pakiety wymienione w pliku, Rozwiązuj i instalując zależności. |
   | Inny typ pliku | Przyjęto, że `.sln` plik jest plikiem, tak jak powyżej; Jeśli nie jest to rozwiązanie, wystąpi błąd. |
   | (nie określono projectPath) | <ul><li>Pakiet NuGet szuka plików rozwiązania w bieżącym folderze. Jeśli zostanie znaleziony pojedynczy plik, jest on używany do przywracania pakietów; Jeśli zostanie znalezionych wiele rozwiązań, wystąpi błąd programu NuGet.</li><li>Jeśli nie ma plików rozwiązania, pakiet NuGet szuka `packages.config` i używa do przywracania pakietów.</li><li>Jeśli nie zostanie znalezione `packages.config` żadne rozwiązanie lub plik, wystąpi błąd programu NuGet.</ul> |

2. Określ folder Packages przy użyciu następującej kolejności priorytetów (NuGet powoduje błąd, jeśli nie odnaleziono żadnego z tych folderów):

    - Folder określony za pomocą `-PackagesDirectory`.
    - `repositoryPath` Wartość w`Nuget.Config`
    - Folder określony za pomocą`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Podczas przywracania pakietów dla rozwiązania NuGet wykonuje następujące czynności:
    - Ładuje plik rozwiązania.
    - Przywraca pakiety na poziomie rozwiązania wymienione `$(SolutionDir)\.nuget\packages.config` w `packages` folderze.
    - Przywróć pakiety wymienione w `$(ProjectDir)\packages.config` `packages` folderze do folderu. Dla każdego określonego pakietu Przywróć pakiet równolegle, chyba że `-DisableParallelProcessing` zostanie określony.

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
