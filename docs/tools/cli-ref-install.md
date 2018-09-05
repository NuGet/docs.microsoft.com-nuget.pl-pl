---
title: Polecenia interfejsu wiersza polecenia NuGet
description: Dokumentacja dla polecenia install nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8261cdb83af72d9d9379124f4c446c7cd2a50299
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549139"
---
# <a name="install-command-nuget-cli"></a>install command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie

Pobiera i instaluje pakiet do projektu, domyślnie używany do bieżącego folderu, za pomocą źródeł określonego pakietu.

> [!Tip]
> Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu na [nuget.org](https://www.nuget.org) i wybierz **Pobierz** łącza.

Jeśli nie określono żadnych źródeł, wymienione w pliku konfiguracji globalnej `%appdata%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), są używane. Zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md) dodatkowe szczegóły.

Jeśli nie określono żadnych określonych pakietów, `install` instaluje wszystkie pakiety wymienione w projekcie `packages.config` pliku, dzięki czemu podobne do [ `restore` ](cli-ref-restore.md).

`install` Polecenie nie modyfikuje plik projektu lub `packages.config`; dzięki temu jest on podobny do `restore` , ponieważ jej tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.

Aby dodać zależność, Dodaj pakiet za pomocą interfejs użytkownika Menedżera pakietów lub konsoli w programie Visual Studio lub zmodyfikować `packages.config` , a następnie uruchom opcję `install` lub `restore`.

## <a name="usage"></a>Użycie

```cli
nuget install <packageID | configFilePath> [options]
```

gdzie `<packageID>` nazwy pakietu do zainstalowania (przy użyciu najnowszej wersji), lub `<configFilePath>` identyfikuje `packages.config` plik, który wyświetla pakiety do zainstalowania. Można wskazać określoną wersję z `-Version` opcji.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| DependencyVersion | *(wersja 4.4 +)*  Wersję pakiety zależności do użycia, które może być jedną z następujących czynności:<br/><ul><li>*Najniższy* (ustawienie domyślne): Najniższa wersja</li><li>*HighestPatch*: wersja przy najniższe główne, najniższą pomocnicza, najwyższy poziom poprawki</li><li>*HighestMinor*: wersji z najniższą główne, najwyższy pomocnicza, najwyższy poziom poprawki</li><li>*Najwyższy*: najwyższa wersja</li></ul> |
| DisableParallelProcessing | Wyłącza równolegle wielu pakietów. |
| ExcludeVersion | Pakiet zostanie zainstalowany w folderze o nazwie nazwę pakietu i nie numer wersji. |
| FallbackSource | *(3.2 +)*  Listę źródeł pakietów do użycia jako przejścia, w przypadku, gdy pakiet nie zostanie odnaleziona w podstawowej lub domyślne źródło. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Framework | *(wersja 4.4 +)*  Docelowa struktura używana do wybierania zależności. Wartość domyślna to "Any" Jeśli nie zostanie określony. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| NoCache | Uniemożliwia korzystania z pamięci podręcznej pakietów NuGet. Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli żaden folder jest określony, używany jest bieżącego folderu. |
| PackageSaveMode | Określa typy plików, aby zapisać po zakończeniu instalacji pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`. |
| Wersja wstępna | Zezwala na pakiety w wersjach wstępnych do zainstalowania. Ta flaga nie jest wymagana podczas przywracania pakietów `packages.config`. |
| RequireConsent | Sprawdza, czy Przywracanie pakietów jest włączona, zanim pobranie i zainstalowanie pakietów. Aby uzyskać więcej informacji, zobacz [Przywracanie pakietów](../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder główny rozwiązania w ramach których można przywrócić pakietów. |
| Źródło | Określa listę źródeł pakietów (jako adresy URL). Jeśli argument jest pominięty, polecenie używa źródeł dostarczane w plikach konfiguracyjnych, zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |
| Wersja | Określa numer wersji pakietu do zainstalowania. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
