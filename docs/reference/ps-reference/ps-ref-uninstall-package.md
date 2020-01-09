---
title: Odinstalowywanie NuGet — Dokumentacja programu PowerShell pakietu
description: Informacje dotyczące polecenia programu PowerShell dotyczącego odinstalowywania pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384418"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem odinstalowywania programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności. Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że określono opcję – Force.

## <a name="syntax"></a>Składnia

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że określono opcję – Force.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | Potrzeb Identyfikator pakietu do odinstalowania. Przełącznik-ID jest opcjonalny. |
| Wersja | Wersja pakietu do odinstalowania, domyślnie przydana do aktualnie zainstalowanej wersji. |
| RemoveDependencies | Odinstaluj pakiet i jego nieużywane zależności. Oznacza to, że jeśli jakakolwiek zależność ma inny pakiet, który od niego zależy, zostanie pominięty. |
| ProjectName | Projekt, z którego ma zostać odinstalowany pakiet, domyślny projekt domyślny. |
| Force | Wymusza odinstalowanie pakietu, nawet jeśli inne pakiety są od niego zależne. |
| Instrukcja WhatIf | Pokazuje, co się stanie po uruchomieniu polecenia bez faktycznego wykonania operacji odinstalowywania. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
