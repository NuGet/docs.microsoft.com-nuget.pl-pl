---
title: Synchronizacja NuGet — Dokumentacja programu PowerShell pakietu
description: Informacje dotyczące polecenia programu PowerShell dla pakietu Sync w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384906"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (konsola menedżera pakietów w programie Visual Studio)

*Wersja 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Pobiera wersję zainstalowanego pakietu z określonego (lub domyślnego) projektu i synchronizuje wersję do pozostałych projektów w rozwiązaniu.

## <a name="syntax"></a>Składnia

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | Potrzeb Identyfikator pakietu do zsynchronizowania. Przełącznik-ID jest opcjonalny. |
| IgnoreDependencies | Zainstaluj tylko ten pakiet, a nie jego zależności. |
| ProjectName | Projekt, z którego ma zostać zsynchronizowany pakiet, domyślnie do projektu domyślnego. |
| Wersja | Wersja pakietu do zsynchronizowania, która domyślnie jest aktualnie zainstalowana wersja. |
| Obiekt źródłowy | Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia `Sync-Package` przeszukuje aktualnie wybrane źródło pakietu. |
| IncludePrerelease | Obejmuje pakiety wersji wstępnej w synchronizacji. |
| FileConflictAction | Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt. Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll*i *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Wersja pakietów zależności do użycia, która może być jedną z następujących:<br/><ul><li>*Najniższy* (domyślny): najniższa wersja</li><li>*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</li><li>*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</li><li>*Najwyższe* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</li></ul>Wartość domyślną można ustawić przy użyciu ustawienia [`dependencyVersion`](../nuget-config-file.md#config-section) w pliku `Nuget.Config`. |
| Instrukcja WhatIf | Pokazuje, co się stanie po uruchomieniu polecenia bez przeprowadzania synchronizacji. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Sync-Package` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

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
