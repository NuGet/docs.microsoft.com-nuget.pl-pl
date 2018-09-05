---
title: Dokumentacja programu PowerShell synchronizacji — pakiet NuGet
description: Dokumentacja poleceń programu PowerShell synchronizacji pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547997"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (konsola menedżera pakietów w programie Visual Studio)

*W wersji 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows.*

Pobiera wersję zainstalowanego pakietu z określony (lub domyślny) projektu i synchronizuje wersji w pozostałej części projektów w rozwiązaniu.

## <a name="syntax"></a>Składnia

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do synchronizacji. — Identyfikator samym przełączniku jest opcjonalne. |
| IgnoreDependencies | Zainstaluj tylko ten pakiet, a nie z jego zależności. |
| ProjectName | Projekt, aby zsynchronizować pakiet, domyślnie używany będzie domyślny projekt. |
| Wersja | Wersja pakietu do synchronizacji, przyjęty obecnie zainstalowanej wersji. |
| Źródło | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu. W przypadku pominięcia `Sync-Package` przeszukuje źródło obecnie wybranego pakietu. |
| IncludePrerelease | Obejmuje pakiety w wersjach wstępnych podczas synchronizacji. |
| FileConflictAction | Akcja do wykonania po wyświetleniu monitu o zastąpienie lub zignorować istniejące pliki przywoływanego przez projekt. Możliwe wartości to *zastąpienia, Zignoruj, None, OverwriteAll*, i *(3.0 i nowsze)* *IgnoreAll*. |
| DependencyVersion | Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:<br/><ul><li>*Najniższy* (ustawienie domyślne): Najniższa wersja</li><li>*HighestPatch*: wersja przy najniższe główne, najniższą pomocnicza, najwyższy poziom poprawki</li><li>*HighestMinor*: wersji z najniższą główne, najwyższy pomocnicza, najwyższy poziom poprawki</li><li>*Najwyższy* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</li></ul>Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ustawienie w `Nuget.Config` pliku. |
| WhatIf | Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania synchronizacji. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Sync-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
