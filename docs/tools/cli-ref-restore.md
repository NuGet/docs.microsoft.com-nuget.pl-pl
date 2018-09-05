---
title: Polecenie restore interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenia restore nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 06e3a26863761b7e7a42752866e7fe369f5be4ef
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550355"
---
# <a name="restore-command-nuget-cli"></a>polecenie Restore (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 2.7 +

Pobiera i instaluje wszystkie pakiety brakuje `packages` folderu. W przypadku użycia za pomocą formatu PackageReference i NuGet 4.0 +, generuje `<project>.nuget.props` pliku, jeśli to konieczne w `obj` folderu. (Plik można pominąć z kontroli źródła.)

W Mac OSX i Linux przy użyciu interfejsu wiersza polecenia na platformy Mono Przywracanie pakietów nie jest obsługiwana przy użyciu funkcji PackageReference.

## <a name="usage"></a>Użycie

```cli
nuget restore <projectPath> [options]
```

gdzie `<projectPath>` Określa lokalizację rozwiązania lub `packages.config` pliku. Zobacz [uwagi](#remarks) poniżej szczegóły zachowania.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| DirectDownload | *(4.0 +)*  Pobiera pakiety bezpośrednio, bez wypełnianie pamięci podręcznych z plików binarnych lub metadanych. |
| DisableParallelProcessing | Wyłącza Przywracanie wielu pakietów równolegle. |
| FallbackSource | *(3.2 +)*  Listę źródeł pakietów do użycia jako przejścia, w przypadku, gdy pakiet nie zostanie odnaleziona w podstawowej lub domyślne źródło. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| MSBuildPath | *(4.0 +)*  Określa ścieżkę program MSBuild będzie używać za pomocą polecenia pierwszeństwo `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Określa numer wersji MSBuild ma być używany za pomocą tego polecenia. Obsługiwane wartości to 4, 12, 14, 15. Domyślnie program MSBuild w ścieżce jest pobierana w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild. |
| NoCache | Uniemożliwia korzystania z pamięci podręcznej pakietów NuGet. Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli żaden folder jest określony, używany jest bieżącego folderu. Wymagana, gdy przywrócenie za pomocą `packages.config` pliku, chyba że `PackagesDirectory` lub `SolutionDirectory` jest używany.|
| PackageSaveMode | Określa typy plików, aby zapisać po zakończeniu instalacji pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`. |
| PackagesDirectory | Taki sam jak `OutputDirectory`. Wymagana, gdy przywrócenie za pomocą `packages.config` pliku, chyba że `OutputDirectory` lub `SolutionDirectory` jest używany. |
| Project2ProjectTimeOut | Przekroczono limit czasu w sekundach dla rozpoznawania odwołania projekt projekt. |
| cykliczne | *(4.0 +)*  Przywraca wszystkie projekty odwołania dla projektów platformy uniwersalnej systemu Windows i platformy .NET Core. Nie ma zastosowania do projektów przy użyciu `packages.config`. |
| RequireConsent | Sprawdza, czy Przywracanie pakietów jest włączona, zanim pobranie i zainstalowanie pakietów. Aby uzyskać więcej informacji, zobacz [Przywracanie pakietów](../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder rozwiązania. Nie jest prawidłowy podczas przywracania pakietów dla rozwiązania. Wymagana, gdy przywrócenie za pomocą `packages.config` pliku, chyba że `PackagesDirectory` lub `OutputDirectory` jest używany. |
| Źródło | Określa listę źródeł pakietów (jako adresy URL) na potrzeby przywracania. Jeśli argument jest pominięty, polecenie używa źródeł dostarczane w plikach konfiguracyjnych, zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md). |
| Szczegółowość |> określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="remarks"></a>Uwagi

Polecenie restore wykonuje następujące czynności:

1. Określ tryb działania polecenia restore.

   | Typ pliku projectPath | Zachowanie |
   | --- | --- |
   | Rozwiązanie (folder) | Wyszukuje NuGet `.sln` pliku i korzysta z jeśli je znaleziono; w przeciwnym razie zwraca błąd. `(SolutionDir)\.nuget` jest używana jako folder początkowy. |
   | `.sln` Plik | Przywróć pakiety identyfikowane za pomocą rozwiązania; Wyświetla błąd, jeśli `-SolutionDirectory` jest używany. `$(SolutionDir)\.nuget` jest używana jako folder początkowy. |
   | `packages.config` lub pliku projektu | Przywróć pakiety wymienione w pliku, rozwiązuje i instalacja zależności. |
   | Inny typ pliku | Plik zakłada się, że `.sln` pliku jako powyżej; Jeśli nie jest rozwiązaniem NuGet zawiera błąd. |
   | (nie określono projectPath) | <ul><li>NuGet szuka plików rozwiązania w bieżącym folderze. Jeśli zostanie znaleziony pojedynczy plik, ten właśnie jest używany w celu przywrócenia pakietów; Jeśli znaleziono wiele rozwiązań NuGet zawiera błąd.</li><li>Jeśli nie ma żadnych plików rozwiązania, NuGet, szuka `packages.config` i użyty do przywrócenia pakietów.</li><li>Jeśli żadne rozwiązanie lub `packages.config` plików zostanie znaleziony, NuGet zawiera błąd.</ul> |

2. Określ folder packages przy użyciu następującej kolejności priorytetu (NuGet powoduje błąd, jeśli nie zostaną znalezione żadne z tych folderów):

    - Folder określony za pomocą `-PackagesDirectory`.
    - `repositoryPath` Back w `Nuget.Config`
    - Folder określony za pomocą `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Trwa przywracanie pakietów rozwiązania, NuGet wykonuje następujące czynności:
    - Ładuje plik rozwiązania.
    - Przywraca pakietów poziomu rozwiązania na liście `$(SolutionDir)\.nuget\packages.config` do `packages` folderu.
    - Przywróć pakiety wymienione w `$(ProjectDir)\packages.config` do `packages` folderu. Dla każdego pakietu jest określony, Przywracanie pakietu w sposób równoległy, chyba że `-DisableParallelProcessing` jest określony.

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
