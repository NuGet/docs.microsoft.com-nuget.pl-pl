---
title: Polecenie przywracania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia przywracania NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8ba61fa87118108c36e9dc73f30d964380d02dab
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380456"
---
# <a name="restore-command-nuget-cli"></a>Restore — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu &bullet; **obsługiwane wersje:** 2.7 +

Pobiera i instaluje wszystkie brakujące pakiety w folderze `packages`. Gdy jest używany z pakietem NuGet 4.0 + i PackageReference, program generuje plik `<project>.nuget.props`, w razie konieczności, w folderze `obj`. (Plik można pominąć z kontroli źródła).

W systemach Mac OSX i Linux przy użyciu interfejsu wiersza polecenia w systemie mono przywracanie pakietów nie jest obsługiwane z PackageReference.

## <a name="usage"></a>Użycie

```cli
nuget restore <projectPath> [options]
```

gdzie `<projectPath>` Określa lokalizację rozwiązania lub plik `packages.config`. Aby uzyskać szczegółowe informacje o zachowaniu, zobacz [uwagi](#remarks) poniżej.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DirectDownload | *(4.0 +)* Pobiera pakiety bezpośrednio bez wypełniania pamięci podręcznych za pomocą jakichkolwiek plików binarnych lub metadanych. |
| DisableParallelProcessing | Wyłącza przywracanie równolegle wielu pakietów. |
| FallbackSource | *(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle. Użyj średnika, aby oddzielić pozycje listy. |
| ForceEnglishOutput | *(3.5 +)* Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| MSBuildPath | *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, która ma pierwszeństwo przed `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild. |
| Nocache | Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Nieinteraktywnych | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie zostanie określony, używany jest bieżący folder. Wymagany w przypadku przywracania z plikiem `packages.config`, chyba że użyto `PackagesDirectory` lub `SolutionDirectory`.|
| PackageSaveMode | Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg` lub `nuspec;nupkg`. |
| PackagesDirectory | Wartość taka sama jak `OutputDirectory`. Wymagany w przypadku przywracania z plikiem `packages.config`, chyba że użyto `OutputDirectory` lub `SolutionDirectory`. |
| Project2ProjectTimeOut | Limit czasu w sekundach dla rozpoznawania odwołań między projektami. |
| rozpoznawania | *(4.0 +)* Przywraca wszystkie projekty odwołań dla projektów platformy UWP i .NET Core. Nie dotyczy projektów korzystających z `packages.config`. |
| RequireConsent | Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów. Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder rozwiązania. Nieprawidłowy podczas przywracania pakietów dla rozwiązania. Wymagany w przypadku przywracania z plikiem `packages.config`, chyba że użyto `PackagesDirectory` lub `OutputDirectory`. |
| Obiekt źródłowy | Określa listę źródeł pakietów (jako adresy URL) do użycia podczas przywracania. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md). Użyj średnika, aby oddzielić pozycje listy. |
| Moc | W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie. Określenie tej flagi jest podobne do usuwania pliku `project.assets.json`. Nie powoduje to obejścia pamięci podręcznej protokołu HTTP. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="remarks"></a>Uwagi

Polecenie Restore wykonuje następujące czynności:

1. Określ tryb operacji przywracania.

   | Typ pliku projectPath | Zachowanie |
   | --- | --- |
   | Rozwiązanie (folder) | Pakiet NuGet szuka pliku `.sln` i używa go, jeśli znaleziono; w przeciwnym razie wystąpi błąd. `(SolutionDir)\.nuget` jest używany jako folder początkowy. |
   | plik `.sln` | Przywróć pakiety zidentyfikowane przez rozwiązanie; występuje błąd, jeśli użyto `-SolutionDirectory`. `$(SolutionDir)\.nuget` jest używany jako folder początkowy. |
   | `packages.config` lub plik projektu | Przywróć pakiety wymienione w pliku, Rozwiązuj i instalując zależności. |
   | Inny typ pliku | Przyjęto, że plik jest plikiem `.sln` jak powyżej; Jeśli nie jest to rozwiązanie, wystąpi błąd programu NuGet. |
   | (nie określono projectPath) | <ul><li>Pakiet NuGet szuka plików rozwiązania w bieżącym folderze. Jeśli zostanie znaleziony pojedynczy plik, jest on używany do przywracania pakietów; Jeśli zostanie znalezionych wiele rozwiązań, wystąpi błąd programu NuGet.</li><li>Jeśli nie ma plików rozwiązania, narzędzie NuGet szuka `packages.config` i używa go do przywracania pakietów.</li><li>Jeśli nie zostanie znaleziony żaden plik rozwiązania lub `packages.config`, pakiet NuGet podaje błąd.</ul> |

2. Określ folder Packages przy użyciu następującej kolejności priorytetów (NuGet powoduje błąd, jeśli nie odnaleziono żadnego z tych folderów):

    - Folder określony za pomocą `-PackagesDirectory`.
    - Wartość `repositoryPath` w `Nuget.Config`
    - Folder określony za pomocą `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Podczas przywracania pakietów dla rozwiązania NuGet wykonuje następujące czynności:
    - Ładuje plik rozwiązania.
    - Przywraca pakiety na poziomie rozwiązania wymienione w `$(SolutionDir)\.nuget\packages.config` do folderu `packages`.
    - Przywróć pakiety wymienione w `$(ProjectDir)\packages.config` do folderu `packages`. Dla każdego określonego pakietu Przywróć pakiet równolegle, chyba że zostanie określony `-DisableParallelProcessing`.

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
