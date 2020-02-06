---
title: Polecenie instalacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia instalacji NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036945"
---
# <a name="install-command-nuget-cli"></a>install command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu &bullet; **obsługiwane wersje:** wszystkie

Pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów.

> [!Tip]
> Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu w witrynie [NuGet.org](https://www.nuget.org) i wybierz link **pobierania** .

Jeśli nie określono żadnych źródeł, używane są wymienione w pliku konfiguracji globalnej, `%appdata%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md) , aby uzyskać dodatkowe informacje.

Jeśli nie określono żadnych określonych pakietów, `install` instaluje wszystkie pakiety wymienione w pliku `packages.config` projektu, co przypomina [`restore`](cli-ref-restore.md).

Polecenie `install` nie modyfikuje pliku projektu ani `packages.config`; w ten sposób przypomina `restore`, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.

Aby dodać zależność, należy dodać pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikować `packages.config` a następnie uruchomić `install` lub `restore`.

## <a name="usage"></a>Użycie

```cli
nuget install <packageID | configFilePath> [options]
```

gdzie `<packageID>` nazywa pakiet, który ma zostać zainstalowany (przy użyciu najnowszej wersji), lub `<configFilePath>` identyfikuje plik `packages.config`, który zawiera listę pakietów do zainstalowania. Możesz wskazać określoną wersję za pomocą opcji `-Version`.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DependencyVersion | *(4.4 +)* Wersja pakietów zależności do użycia, która może być jedną z następujących:<br/><ul><li>*Najniższy* (domyślny): najniższa wersja</li><li>*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</li><li>*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</li><li>*Najwyższa*: najwyższa wersja</li><li>*Ignoruj*: nie będą używane żadne pakiety zależności</li></ul> |
| DisableParallelProcessing | Wyłącza równoczesne Instalowanie wielu pakietów. |
| ExcludeVersion | Instaluje pakiet w folderze o nazwie tylko w nazwie pakietu, a nie w numerze wersji. |
| FallbackSource | *(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle. |
| ForceEnglishOutput | *(3.5 +)* Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| Framework | *(4.4 +)* Platforma docelowa używana do wybierania zależności. Jeśli nie zostanie określony, wartością domyślną będzie "any". |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| NoCache | Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie zostanie określony, używany jest bieżący folder. |
| PackageSaveMode | Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`lub `nuspec;nupkg`. |
| PreRelease | Zezwala na zainstalowanie pakietów wersji wstępnej. Ta flaga nie jest wymagana podczas przywracania pakietów z `packages.config`. |
| RequireConsent | Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów. Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder główny rozwiązania, dla którego mają zostać przywrócone pakiety. |
| Źródło | Określa listę źródeł pakietów (jako adresy URL) do użycia. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |
| Wersja | Określa wersję pakietu do zainstalowania. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
