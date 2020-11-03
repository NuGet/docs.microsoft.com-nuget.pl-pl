---
title: Dokumentacja programu NuGet Uninstall-Package PowerShell
description: Informacje dotyczące Uninstall-Package polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237130"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konsola Menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Ogólne polecenie programu PowerShell Uninstall-Package można znaleźć w [dokumentacji programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

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

`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```