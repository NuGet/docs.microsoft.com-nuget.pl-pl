---
title: Dokumentacja programu NuGet Get-Project PowerShell
description: Odwołanie do polecenia getproject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238078"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Wyświetla informacje dotyczące domyślnego lub określonego projektu. `Get-Project` w odniesieniu do obiektu "Visual Studio DTE (środowisko narzędzi programistycznych)" zwraca referent.

## <a name="syntax"></a>Składnia

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Nazwa | Określa projekt do wyświetlenia, domyślny projekt domyślny wybrany w konsoli Menedżera pakietów. Przełącznik-Name jest opcjonalny. |
| Wszystko | Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Get-Project` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```