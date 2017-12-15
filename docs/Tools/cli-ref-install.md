---
title: Polecenie instalowania NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: Dokumentacja dla polecenia install nuget.exe
keywords: "nuget zainstalować odwołania, należy zainstalować pakiet polecenia"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>Zainstaluj polecenia (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie

Pobiera i instaluje pakiet w projekcie, domyślnie używany do bieżącego folderu przy użyciu określonego pakietu źródeł.

> [!Tip]
> Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu na [nuget.org](https://www.nuget.org) i wybierz **Pobierz** łącza. 

Jeśli nie określono żadnych źródeł, wymienione w pliku konfigurację globalną `%APPDATA%\NuGet\NuGet.Config`, są używane. Zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md) dodatkowe szczegóły.

Jeśli nie określono żadnych określonych pakietów, `install` instaluje wszystkie pakiety wymienione w projekcie `packages.config` plików, dzięki czemu podobny do [ `restore` ](#restore). ( `install` Nie obsługuje polecenia `project.json`.)

`install` Polecenia nie modyfikuje plik projektu lub `packages.config`; w ten sposób jest podobna do `restore` w tym go tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.

Aby dodać zależność, Dodaj projekt za pomocą Menedżera pakietów interfejsu użytkownika lub konsoli w programie Visual Studio lub zmodyfikować `packages.config` , a następnie uruchom albo `install` lub `restore`. Dla projektów przy użyciu `project.json`, można modyfikować tego pliku, a następnie uruchom `restore`.

## <a name="usage"></a>Użycie

```
nuget install <packageID | configFilePath> [options]
```

gdzie `<packageID>` nazwy pakietu do zainstalowania (przy użyciu najnowszej wersji,) lub `<configFilePath>` identyfikuje `packages.config` plik zawierający listę pakietów do zainstalowania. Można wskazać określoną wersję z `-Version` opcji.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | *(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| DisableParallelProcessing | Wyłącza równolegle wielu pakietów. |
| ExcludeVersion | Instaluje pakiet do folderu o nazwie z tylko nazwę pakietu i nie numer wersji. |
| FallbackSource | *(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Framework | *(4.4 +)*  Platformy docelowej służy do wybierania zależności. Wartość domyślna to "Any" Jeśli nie zostanie określony. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| NoCache | Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie jest określony, używany jest bieżący folder. |
| PackageSaveMode | Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`. |
| Wydanie wstępne | Zezwala na pakiety wersji wstępnej do zainstalowania. Ta flaga nie jest wymagana, gdy trwa przywracanie pakietów z `packages.config`. |
| RequireConsent | Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów. Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder główny rozwiązaniu, dla których pod kątem przywracania pakietów. |
| Źródło | Określa listę źródła pakietu (jako adresy URL). W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |
| Wersja | Określa wersję pakietu do zainstalowania. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
