---
title: Polecenie instalacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia instalacji NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328340"
---
# <a name="install-command-nuget-cli"></a>install command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : wszystkie

Pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów.

> [!Tip]
> Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu w witrynie [NuGet.org](https://www.nuget.org) i wybierz link **pobierania** .

Jeśli nie określono żadnych źródeł, są używane wymienione w pliku `%appdata%\NuGet\NuGet.Config` konfiguracji globalnej (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md) , aby uzyskać dodatkowe informacje.

Jeśli nie określono żadnych określonych pakietów, `install` program zainstaluje wszystkie pakiety wymienione w `packages.config` pliku projektu [`restore`](cli-ref-restore.md), co przypomina.

Polecenie nie modyfikuje pliku projektu lub `packages.config`; w ten sposób jest podobne do `restore` programu, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu. `install`

Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj `packages.config` , a następnie uruchom `restore`albo `install` .

## <a name="usage"></a>Użycie

```cli
nuget install <packageID | configFilePath> [options]
```

gdzie `<packageID>` nazywa pakiet, który ma zostać zainstalowany (przy użyciu najnowszej wersji) `<configFilePath>` , lub `packages.config` identyfikuje plik, który zawiera listę pakietów do zainstalowania. Można wskazać określoną wersję z `-Version` opcją.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| DependencyVersion | *(4.4 +)* Wersja pakietów zależności do użycia, która może być jedną z następujących:<br/><ul><li>*Najniższy* (domyślnie): najniższa wersja</li><li>*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</li><li>*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</li><li>*Najwyższa*: najwyższa wersja</li></ul> |
| DisableParallelProcessing | Wyłącza równoczesne Instalowanie wielu pakietów. |
| ExcludeVersion | Instaluje pakiet w folderze o nazwie tylko w nazwie pakietu, a nie w numerze wersji. |
| FallbackSource | *(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Framework | *(4.4 +)* Platforma docelowa używana do wybierania zależności. Jeśli nie zostanie określony, wartością domyślną będzie "any". |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NoCache | Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie zostanie określony, używany jest bieżący folder. |
| PackageSaveMode | Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`lub `nuspec;nupkg`. |
| Wersja wstępna | Zezwala na zainstalowanie pakietów wersji wstępnej. Ta flaga nie jest wymagana podczas przywracania pakietów przy `packages.config`użyciu programu. |
| RequireConsent | Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów. Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder główny rozwiązania, dla którego mają zostać przywrócone pakiety. |
| Source | Określa listę źródeł pakietów (jako adresy URL) do użycia. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |
| Wersja | Określa wersję pakietu do zainstalowania. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
