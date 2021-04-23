---
title: Informacje o programie PowerShell Uninstall-Package NuGet
description: Informacje dotyczące Uninstall-Package programu PowerShell w konsoli Menedżer pakietów NuGet w Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901788"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Menedżer pakietów Console in Visual Studio)

*W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie polecenia Uninstall-Package PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell](/powershell/module/packagemanagement).*

Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności. Jeśli inne pakiety zależą od tego pakietu, polecenie nie powiedzie się, chyba że określono opcję –Force.

## <a name="syntax"></a>Składnia

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Jeśli inne pakiety zależą od tego pakietu, polecenie nie powiedzie się, chyba że określono opcję –Force.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do odinstalowania. Sam przełącznik -Id jest opcjonalny. |
| Wersja | Wersja pakietu do odinstalowania, domyślnie zainstalowana wersja. |
| RemoveDependencies | Odinstaluj pakiet i jego nieużywane zależności. Oznacza to, że jeśli jakakolwiek zależność ma inny pakiet, który od niego zależy, zostanie pominięty. |
| ProjectName | Projekt, z którego ma zostać odinstalowany pakiet ( domyślnie jest to projekt domyślny). |
| Force | Wymusza odinstalowanie pakietu, nawet jeśli od niego zależą inne pakiety. |
| Instrukcja WhatIf | Pokazuje, co się stanie w przypadku uruchomienia polecenia bez przeprowadzania dezinstalacji. |

Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Typowe parametry

`Uninstall-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```