---
title: Dokumentacja programu PowerShell Install pakiet NuGet
description: Dokumentacja poleceń programu PowerShell Install-Package, w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546029"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia programu PowerShell Install-Package, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Instaluje pakiet i jego zależności do projektu.

## <a name="syntax"></a>Składnia

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

W pakiecie NuGet 2.8 + `Install-Package` mogą obniżyć wersję istniejącego pakietu w projekcie. Na przykład w przypadku 5.1.0-rc1 Microsoft.AspNet.MVC zainstalowane następujące polecenie będzie obniżyć do 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do zainstalowania. (*3.0 +*) identyfikator może być ścieżka lub adres URL `packages.config` pliku lub `.nupkg` pliku. — Identyfikator samym przełączniku jest opcjonalne. |
| IgnoreDependencies | Zainstaluj tylko ten pakiet, a nie z jego zależności. |
| ProjectName | Projekt, do którego można zainstalować pakietu, domyślnie używany będzie domyślny projekt. |
| Źródło | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu. W przypadku pominięcia `Install-Package` przeszukuje źródło obecnie wybranego pakietu. |
| Wersja | Wersja pakietu do zainstalowania, ustawiając domyślnie do najnowszej wersji. |
| IncludePrerelease | Uwzględnia pakiety w wersjach wstępnych instalacji. Jeśli argument jest pominięty, są traktowane jako tylko stabilne pakiety. |
| FileConflictAction | Akcja do wykonania po wyświetleniu monitu o zastąpienie lub zignorować istniejące pliki przywoływanego przez projekt. Możliwe wartości to *zastąpienia, Zignoruj, None, OverwriteAll*, i *(3.0 i nowsze)* *IgnoreAll*. |
| DependencyVersion | Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:<br/><ul><li>*Najniższy* (ustawienie domyślne): Najniższa wersja</li><li>*HighestPatch*: wersja przy najniższe główne, najniższą pomocnicza, najwyższy poziom poprawki</li><li>*HighestMinor*: wersji z najniższą główne, najwyższy pomocnicza, najwyższy poziom poprawki</li><li>*Najwyższy* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</li></ul>Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ustawienie w `Nuget.Config` pliku. |
| WhatIf | Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania instalacji. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Install-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

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
