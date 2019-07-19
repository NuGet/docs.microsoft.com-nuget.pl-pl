---
title: Instalacja NuGet — Dokumentacja programu PowerShell pakietu
description: Informacje dotyczące polecenia install-package programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328205"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem install-package programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Instaluje pakiet i jego zależności w projekcie.

## <a name="syntax"></a>Składnia

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

W programie NuGet 2.8 + `Install-Package` można obniżyć poziom istniejącego pakietu w projekcie. Na przykład jeśli masz zainstalowany plik Microsoft. AspNet. MVC 5.1.0-RC1, następujące polecenie obniży go do 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | Potrzeb Identyfikator pakietu do zainstalowania. (*3.0 +* ) Identyfikator może być ścieżką lub adresem URL `packages.config` pliku `.nupkg` lub pliku. Przełącznik-ID jest opcjonalny. |
| IgnoreDependencies | Zainstaluj tylko ten pakiet, a nie jego zależności. |
| ProjectName | Projekt, w którym ma zostać zainstalowany pakiet, domyślny dla projektu domyślnego. |
| Source | Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia program `Install-Package` przeszukuje aktualnie wybrane źródło pakietu. |
| Wersja | Wersja pakietu do zainstalowania, domyślnie przyaktualna do najnowszej wersji. |
| IncludePrerelease | Traktuje pakiety wersji wstępnej do zainstalowania. W przypadku pominięcia są brane pod uwagę tylko pakiety stabilne. |
| FileConflictAction | Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt. Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll*i *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Wersja pakietów zależności do użycia, która może być jedną z następujących:<br/><ul><li>*Najniższy* (domyślnie): najniższa wersja</li><li>*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</li><li>*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</li><li>*Najwyższa* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</li></ul>Możesz ustawić wartość domyślną przy użyciu [`dependencyVersion`](../nuget-config-file.md#config-section) ustawienia `Nuget.Config` w pliku. |
| WhatIf | Pokazuje, co się stanie po uruchomieniu polecenia bez faktycznego wykonania instalacji. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Install-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
