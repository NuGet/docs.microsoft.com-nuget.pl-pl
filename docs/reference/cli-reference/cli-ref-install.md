---
title: Polecenie instalacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia instalacji nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623100"
---
# <a name="install-command-nuget-cli"></a>Install — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: wszystkie

Pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów.

> [!Tip]
> Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu w witrynie [NuGet.org](https://www.nuget.org) i wybierz link **pobierania** .

Jeśli nie określono żadnych źródeł, są używane wymienione w pliku konfiguracji globalnej `%appdata%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md) , aby uzyskać dodatkowe informacje.

Jeśli nie określono żadnych określonych pakietów, program `install` zainstaluje wszystkie pakiety wymienione w `packages.config` pliku projektu, co przypomina [`restore`](cli-ref-restore.md) .

`install`Polecenie nie modyfikuje pliku projektu lub `packages.config` ; w ten sposób jest podobne do `restore` programu, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.

Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj, `packages.config` a następnie uruchom albo `install` `restore` .

## <a name="usage"></a>Użycie

```cli
nuget install <packageID | configFilePath> [options]
```

gdzie `<packageID>` nazywa pakiet, który ma zostać zainstalowany (przy użyciu najnowszej wersji), lub `<configFilePath>` identyfikuje `packages.config` plik, który zawiera listę pakietów do zainstalowania. Można wskazać określoną wersję z `-Version` opcją.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-DependencyVersion`**

  *(4.4 +)* Wersja pakietów zależności do użycia, która może być jedną z następujących:<br/><ul><li>*Najniższy* (domyślny): najniższa wersja</li><li>*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</li><li>*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</li><li>*Najwyższa*: najwyższa wersja</li><li>*Ignoruj*: nie będą używane żadne pakiety zależności</li></ul>

- **`-DirectDownload`**

  Pobierz bezpośrednio bez wypełniania pamięci podręcznych za pomocą metadanych lub plików binarnych.

- **`-DisableParallelProcessing`**

  Wyłącza równoczesne Instalowanie wielu pakietów.

- **`-x|-ExcludeVersion`**

  Instaluje pakiet w folderze o nazwie tylko w nazwie pakietu, a nie w numerze wersji.

- **`-FallbackSource`**

  *(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-Framework`**

  *(4.4 +)* Platforma docelowa używana do wybierania zależności. Jeśli nie zostanie określony, wartością domyślną będzie "any".

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NoCache`**

  Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-OutputDirectory`**

  Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie zostanie określony, używany jest bieżący folder.

- **`-PackageSaveMode`**

  Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec` , `nupkg` lub `nuspec;nupkg` .

- **`-PreRelease`**

  Zezwala na zainstalowanie pakietów wersji wstępnej. Ta flaga nie jest wymagana podczas przywracania pakietów przy użyciu programu `packages.config` .

- **`-RequireConsent`**

  Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów. Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Określa folder główny rozwiązania, dla którego mają zostać przywrócone pakiety.

- **`-Source`**

   Określa listę źródeł pakietów (jako adresy URL) do użycia. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

- **`-Version`**

  Określa wersję pakietu do zainstalowania.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
