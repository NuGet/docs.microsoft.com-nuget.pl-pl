---
title: Dokumentacja programu PowerShell odinstalować — pakiet NuGet
description: Dokumentacja polecenia PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551646"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia pakietu dezinstalacji programu PowerShell, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Usuwa pakiet z projektem, opcjonalnie usunięcie jego zależności. Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że Force określono opcję.

## <a name="syntax"></a>Składnia

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że Force określono opcję.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do odinstalowania. — Identyfikator samym przełączniku jest opcjonalne. |
| Wersja | Wersja pakietu, aby odinstalować, przyjęty obecnie zainstalowanej wersji. |
| RemoveDependencies | Odinstaluj pakiet i jego zależności nieużywane. Oznacza to jeśli wszystkie zależności ma inny pakiet, który zależy od niego, zostanie ona pominięta. |
| ProjectName | Projekt, z którego można odinstalować pakietu, domyślnie używany będzie domyślny projekt. |
| Wymuś | Wymusza pakietu dezinstalację, nawet jeśli inne pakiety są od niego zależne. |
| WhatIf | Pokazuje, co się stanie, podczas uruchamiania polecenia bez rzeczywistego wykonania dezinstalacji. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
