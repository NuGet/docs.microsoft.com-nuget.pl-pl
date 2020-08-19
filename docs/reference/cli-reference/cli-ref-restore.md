---
title: Polecenie przywracania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia Restore
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622833"
---
# <a name="restore-command-nuget-cli"></a>Restore — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: 2.7 +

Pobiera i instaluje wszystkie brakujące pakiety w `packages` folderze. W przypadku użycia z pakietem NuGet 4.0 + i formatem PackageReference program generuje `<project>.nuget.props` plik, w razie konieczności, w `obj` folderze. (Plik można pominąć z kontroli źródła).

W systemach Mac OSX i Linux przy użyciu interfejsu wiersza polecenia w systemie mono przywracanie pakietów nie jest obsługiwane z PackageReference.

## <a name="usage"></a>Użycie

```cli
nuget restore <projectPath> [options]
```

gdzie `<projectPath>` określa lokalizację rozwiązania lub `packages.config` pliku. Aby uzyskać szczegółowe informacje o zachowaniu, zobacz [uwagi](#remarks) poniżej.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-DirectDownload`**

  *(4.0 +)* Pobiera pakiety bezpośrednio bez wypełniania pamięci podręcznych za pomocą jakichkolwiek plików binarnych lub metadanych.

- **`-DisableParallelProcessing`**

   Wyłącza przywracanie równolegle wielu pakietów.

- **`-FallbackSource`**

  *(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle. Użyj średnika, aby oddzielić pozycje listy.

- **`-Force`**

  W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie. Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku. Nie powoduje to obejścia pamięci podręcznej protokołu HTTP.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-ForceEvaluate`**

  Wymusza przywrócenie przez Przywracanie wszystkich zależności, nawet jeśli plik blokady już istnieje.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-LockFilePath`**

  Lokalizacja wyjściowa, w której jest zapisywana plik blokady projektu. Domyślnie jest to `PROJECT_ROOT\packages.lock.json` .

- **`-LockedMode`**

  Nie Zezwalaj na aktualizowanie pliku blokady projektu.

- **`-MSBuildPath`**

   *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo przed `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.

- **`-NoCache`**

  Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-OutputDirectory`**

  Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie zostanie określony, używany jest bieżący folder. Wymagane w przypadku przywracania z `packages.config` plikiem, chyba że `PackagesDirectory` lub `SolutionDirectory` jest używany.

- **`-PackageSaveMode`**

  Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec` , `nupkg` lub `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Analogicznie jak `OutputDirectory` . Wymagane w przypadku przywracania z `packages.config` plikiem, chyba że `OutputDirectory` lub `SolutionDirectory` jest używany.

- **`-Project2ProjectTimeOut`**

  Limit czasu w sekundach dla rozpoznawania odwołań między projektami.

- **`-Recursive`**

  *(4.0 +)* Przywraca wszystkie projekty odwołań dla projektów platformy UWP i .NET Core. Nie dotyczy projektów korzystających z programu `packages.config` .

- **`-RequireConsent`**

  Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów. Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Określa folder rozwiązania. Nieprawidłowy podczas przywracania pakietów dla rozwiązania. Wymagane w przypadku przywracania z `packages.config` plikiem, chyba że `PackagesDirectory` lub `OutputDirectory` jest używany.

- **`-Source`**

  Określa listę źródeł pakietów (jako adresy URL) do użycia podczas przywracania. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md). Użyj średnika, aby oddzielić pozycje listy.

- **`-UseLockFile`**

  Umożliwia generowanie i używanie pliku blokady projektu z przywracaniem.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="remarks"></a>Uwagi

Polecenie Restore wykonuje następujące czynności:

1. Określ tryb operacji przywracania.

   | Typ pliku projectPath | Zachowanie |
   | --- | --- |
   | Rozwiązanie (folder) | Pakiet NuGet szuka `.sln` pliku i używa go, jeśli został znaleziony; w przeciwnym razie wystąpi błąd. `(SolutionDir)\.nuget` jest używany jako folder początkowy. |
   | `.sln` rozszerzeniem | Przywróć pakiety zidentyfikowane przez rozwiązanie; występuje błąd, jeśli `-SolutionDirectory` jest używany. `$(SolutionDir)\.nuget` jest używany jako folder początkowy. |
   | `packages.config` lub plik projektu | Przywróć pakiety wymienione w pliku, Rozwiązuj i instalując zależności. |
   | Inny typ pliku | Przyjęto, że plik jest `.sln` plikiem, tak jak powyżej; Jeśli nie jest to rozwiązanie, wystąpi błąd. |
   | (nie określono projectPath) | <ul><li>Pakiet NuGet szuka plików rozwiązania w bieżącym folderze. Jeśli zostanie znaleziony pojedynczy plik, jest on używany do przywracania pakietów; Jeśli zostanie znalezionych wiele rozwiązań, wystąpi błąd programu NuGet.</li><li>Jeśli nie ma plików rozwiązania, pakiet NuGet szuka `packages.config` i używa do przywracania pakietów.</li><li>Jeśli nie zostanie znalezione żadne rozwiązanie lub `packages.config` plik, wystąpi błąd programu NuGet.</ul> |

2. Określ folder Packages przy użyciu następującej kolejności priorytetów (NuGet powoduje błąd, jeśli nie odnaleziono żadnego z tych folderów):

    - Folder określony za pomocą `-PackagesDirectory` .
    - `repositoryPath`Wartość w`Nuget.Config`
    - Folder określony za pomocą `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Podczas przywracania pakietów dla rozwiązania NuGet wykonuje następujące czynności:
    - Ładuje plik rozwiązania.
    - Przywraca pakiety na poziomie rozwiązania wymienione w `$(SolutionDir)\.nuget\packages.config` `packages` folderze.
    - Przywróć pakiety wymienione w `$(ProjectDir)\packages.config` folderze do `packages` folderu. Dla każdego określonego pakietu Przywróć pakiet równolegle, chyba że `-DisableParallelProcessing` zostanie określony.

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
