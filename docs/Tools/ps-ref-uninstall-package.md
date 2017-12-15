---
title: "Odinstaluj — pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Odwołanie do polecenia programu PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, odinstaluj pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Odinstaluj pakiet (Konsola Menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakietu dezinstalacji programu PowerShell, zobacz [odwołania programu PowerShell PackageManagement](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*

Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności. Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.

## <a name="syntax"></a>Składnia

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Identyfikator | (Wymagane) Identyfikator pakietu do odinstalowania. Id przełącznika sam jest opcjonalna. |
| Wersja | Wersja pakietu do odinstalowania, przyjęty obecnie zainstalowanej wersji. |
| RemoveDependencies | Odinstaluj pakiet i jego nieużywane zależności. Oznacza to jeśli wszystkie zależności zależy od niego inny pakiet, zostaje pominięta. |
| ProjectName | Projekt, z którego ma zostać odinstalowany pakiet, domyślnie używany do projektu domyślnego. |
| Wymuś | Wymusza pakietu do odinstalowania, nawet jeśli inne pakiety są od niego zależne. |
| Instrukcja WhatIf | Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania dezinstalacji. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Uninstall-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
