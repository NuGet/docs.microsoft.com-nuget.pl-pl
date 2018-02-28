---
title: Zainstaluj pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Odwołanie do polecenia programu PowerShell Install-Package w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Install-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f5f6b3dffb27af510b750650561cdff597c927e0
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Konsola Menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Polecenia programu PowerShell Install-Package ogólny, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Instaluje pakiet i jego zależności w projekcie.

## <a name="syntax"></a>Składnia

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

W NuGet 2.8 + `Install-Package` mogłoby obniżyć poziom istniejącego pakietu w projekcie. Na przykład jeśli masz zainstalowany 5.1.0-rc1 Microsoft.AspNet.MVC następujące polecenie spowoduje obniżyć go 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

NuGet 2.7 i starszych zwraca błąd informujący o tym, że jest już zainstalowana nowsza wersja.
  
## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do zainstalowania. (*3.0 +*) identyfikator może być ścieżka lub adres URL `packages.config` pliku lub `.nupkg` pliku. Id przełącznika sam jest opcjonalna. |
| IgnoreDependencies | Zainstaluj tylko ten pakiet, bez jego zależności. |
| ProjectName | Projekt, do którego można zainstalować pakietu, domyślnie używany do projektu domyślnego. |
| Źródło | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu. Pominięcie `Install-Package` wyszukiwania w obecnie wybranym źródle pakietów. |
| Wersja | Wersja pakietu do zainstalowania, domyślnie używany do najnowszej wersji. |
| IncludePrerelease | Uwzględnia pakiety wersji wstępnej instalacji. W przypadku jego pominięcia są traktowane jako tylko pakiety w wersji stabilnej. |
| FileConflictAction | Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt. Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:<br/><ul><li>*Najniższa* (domyślnie): Najniższa wersja</li><li>*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</li><li>*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</li><li>*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</li></ul>Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` pliku. |
| WhatIf | Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania instalacji. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Install-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
