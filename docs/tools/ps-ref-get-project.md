---
title: Get projekt NuGet w programie PowerShell
description: Odwołanie do polecenia programu GetProject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817759"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (konsola menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*

Wyświetla informacje o domyślnych lub określony projekt. `Get-Project` w szczególności zwraca obiekt obsługujący w obiekt Visual Studio DTE (Development Tools Environment) dla projektu.

## <a name="syntax"></a>Składnia

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Nazwa | Określa projekt do wyświetlenia, domyślnie używany będzie domyślny projekt wybrany w konsoli Menedżera pakietów. -Name przełącznik jest opcjonalne. |
| Wszystkie | Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Get-Project` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```