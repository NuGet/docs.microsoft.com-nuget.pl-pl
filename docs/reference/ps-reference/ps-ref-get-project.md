---
title: Dokumentacja pakietu NuGet Get-Project PowerShell
description: Odwołanie do polecenia getproject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328211"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (konsola menedżera pakietów w programie Visual Studio)

*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Wyświetla informacje dotyczące domyślnego lub określonego projektu. `Get-Project`w odniesieniu do obiektu "Visual Studio DTE (środowisko narzędzi programistycznych)" zwraca referent.

## <a name="syntax"></a>Składnia

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Nazwa | Określa projekt do wyświetlenia, domyślny projekt domyślny wybrany w konsoli Menedżera pakietów. Przełącznik-Name jest opcjonalny. |
| Wszystkie | Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Get-Project`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```